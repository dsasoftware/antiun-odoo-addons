CRM Sector
==========

Addon divided into OCA/crm/crm_sector and OCA/partner-contact/partner_sector.

Before updating database:

ALTER TABLE crm_sector RENAME TO res_partner_sector;
ALTER SEQUENCE crm_sector_id_seq RENAME TO res_partner_sector_id_seq;
ALTER INDEX crm_sector_pkey RENAME TO res_partner_sector_pkey;
ALTER INDEX crm_sector_parent_left_index RENAME TO res_partner_sector_parent_left_index;
ALTER INDEX crm_sector_parent_right_index RENAME TO res_partner_sector_parent_right_index;
ALTER TABLE res_partner_sector RENAME CONSTRAINT crm_sector_create_uid_fkey TO res_partner_sector_create_uid_fkey;
ALTER TABLE res_partner_sector RENAME CONSTRAINT crm_sector_parent_id_fkey TO res_partner_sector_parent_id_fkey;
ALTER TABLE res_partner_sector RENAME CONSTRAINT crm_sector_write_uid_fkey TO res_partner_sector_write_uid_fkey;
ALTER TABLE crm_lead_crm_sector_rel RENAME TO crm_lead_res_partner_sector_rel;
ALTER TABLE crm_lead_res_partner_sector_rel RENAME COLUMN crm_sector_id TO res_partner_sector_id;
ALTER INDEX crm_lead_crm_sector_rel_crm_lead_id_crm_sector_id_key RENAME TO crm_lead_res_partner_sector_r_crm_lead_id_res_partner_secto_key;
ALTER INDEX crm_lead_crm_sector_rel_crm_lead_id_index RENAME TO crm_lead_res_partner_sector_rel_crm_lead_id_index;
ALTER INDEX crm_lead_crm_sector_rel_crm_sector_id_index RENAME TO crm_lead_res_partner_sector_rel_res_partner_sector_id_index;
ALTER TABLE crm_lead_res_partner_sector_rel RENAME CONSTRAINT crm_lead_crm_sector_rel_crm_lead_id_fkey TO crm_lead_res_partner_sector_rel_crm_lead_id_fkey;
ALTER TABLE crm_lead_res_partner_sector_rel RENAME CONSTRAINT crm_lead_crm_sector_rel_crm_sector_id_fkey TO crm_lead_res_partner_sector_rel_res_partner_sector_id_fkey;
ALTER TABLE crm_sector_res_partner_rel RENAME TO res_partner_res_partner_sector_rel;
ALTER TABLE res_partner_res_partner_sector_rel RENAME COLUMN crm_sector_id TO res_partner_sector_id;
ALTER INDEX crm_sector_res_partner_rel_res_partner_id_crm_sector_id_key RENAME TO res_partner_res_partner_secto_res_partner_id_res_partner_se_key;
ALTER INDEX crm_sector_res_partner_rel_crm_sector_id_index RENAME TO res_partner_res_partner_sector_rel_res_partner_sector_id_index;
ALTER INDEX crm_sector_res_partner_rel_res_partner_id_index RENAME TO res_partner_res_partner_sector_rel_res_partner_id_index;
ALTER TABLE res_partner_res_partner_sector_rel RENAME CONSTRAINT crm_sector_res_partner_rel_crm_sector_id_fkey TO res_partner_res_partner_sector_rel_res_partner_sector_id_fkey;
ALTER TABLE res_partner_res_partner_sector_rel RENAME CONSTRAINT crm_sector_res_partner_rel_res_partner_id_fkey TO res_partner_res_partner_sector_rel_res_partner_id_fkey;
UPDATE ir_translation set name = 'res.partner.sector,name' where name = 'crm.sector,name' and type = 'model';
ALTER TABLE res_partner RENAME COLUMN sector to sector_id;
ALTER TABLE res_partner RENAME CONSTRAINT res_partner_sector_fkey to res_partner_sector_id_fkey;
ALTER TABLE crm_lead RENAME COLUMN sector to sector_id;
ALTER TABLE crm_lead RENAME CONSTRAINT crm_lead_sector_fkey to crm_lead_sector_id_fkey;
DELETE FROM ir_ui_view WHERE id IN (SELECT id FROM ir_ui_view WHERE arch LIKE '%name="sector"%');
